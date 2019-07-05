# FSM
Finite State Machine


      module vending(out,coin,clk,rst);
        output reg out;
        input [1:0] coin;
        input       clk,rst;

        reg [1:0]   state,next_state;

        parameter s0=2'd0,
           s5=2'd1,
           s10=2'd2,
           s15=2'd3;

        parameter x0=2'd0,
           x5=2'd1,
           x10=2'd2,
           x15=2'd3;

        always @ (posedge clk)
           begin
            if(rst)
            state=s0;
                else
            state=next_state;
           end

      always @ (state,coin)
          begin
            case(state)

          s0:begin
            if(coin==x5)
            begin
            next_state=s5;
            out=0;
            end
         
          else if(coin==x0)
            begin
            next_state=s0;
            out=0;
            end
         
          else if(coin==x10)
            begin
            next_state=s10;
            out=0;
            end
          end // case: s0

          s5:begin
            if(coin==x0)
            begin
            next_state=s5;
            out=0;
            end
         else if(coin==x5)
            begin
            next_state=x10;
            out=0;
            end
         else if(coin==x10)
            begin
            next_state=s15;
            out=0;
            end
         end // case: s5

          s10:begin
            if(coin==x0)
            begin
            next_state=s10;
            out=0;
            end
          else if(coin==x5)
            begin
            next_state=x15;
            out=0;
            end
          else if(coin==x10)
            begin
            next_state=s15;
            out=0;
            end
          end // case: s10

          s15:
            begin
            out=1;
            next_state=s0;
            end
            endcase
          end // always @ (state,coin)
    endmodule // vending
